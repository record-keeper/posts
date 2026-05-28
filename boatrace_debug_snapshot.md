# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-28T15:40:02.154872+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×42 (24h)
- 🔴 PSI_DRIFT_DETECTED×36 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 KS_ODDS_DRIFT  ×13  [2026-05-28T15:27:23]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🔴 CIRCUIT_BREAKER_TRIP  ×36  [2026-05-28T15:04:34]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×36  [2026-05-28T15:04:34]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×36  [2026-05-28T15:04:34]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×36  [2026-05-28T15:04:34]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-05-28T15:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×50  [2026-05-28T13:21:08]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×5  [2026-05-28T13:17:22]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-05-28T10:00:09]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-28T06:00:24]
- key: `INSUFFICIENT_SAMPLE|S00: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-28T06:00:24]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=26 pred=0.3234 actual=0.2308 gap=+0.0926`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-28T06:00:24]
- key: `DRIFT_BUCKET|drift ≥+30%: n=35 hit%=20.0% ROI=0.57 (コスト 9,000/回収 5,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-28T06:00:24]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-28T06:00:24]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1957 actual=0.2000 gap=-0.0043`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-28T06:00:24]
- key: `ROI_STAT|S01_NAKAANA1: n=83 hit%=28.9% hit_CI[Bonf]=[17.0,44.7]% ROI=0.77 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-28T06:00:24]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=83<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-28T06:00:24]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=83 pred=0.4839 hit=0.2892 cal_err=+0.1947 brier=0.2471 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-28T06:00:24]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=12 pred=0.2234 actual=0.4167 gap=-0.1933`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-28T06:00:24]
- key: `CALIBRATION_LIVE|decile 0.50+: n=144 pred=0.5400 actual=0.3750 gap=+0.1650`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-28T06:00:24]
- key: `ROI_STAT|S00: n=176 hit%=29.0% hit_CI[Bonf]=[20.2,39.6]% ROI=0.97 ROI_boot95=[0.73,1.28]`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.61MB / last modified 2026-05-28T15:39:06.393768+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
arsed
2026-05-28 15:37:20,603 [INFO] scraper: odds2t: 30/30 parsed
2026-05-28 15:37:20,604 [INFO] scraper: odds2f: 14/15 parsed
2026-05-28 15:37:21,710 [INFO] scraper: odds_win: 3/6 parsed
2026-05-28 15:37:21,711 [INFO] scraper: fetch_race 08/12: boats=6 odds=187/191
2026-05-28 15:37:21,714 [INFO] predictor: CALIBRATION_MODE=on
2026-05-28 15:37:21,714 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-05-28 15:37:21,718 [INFO] run_cycle: fetched 08/12 [scan]: 153 combos
2026-05-28 15:37:21,820 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-28 15:38:05,760 [INFO] run_cycle: === run_cycle 15:38:05 ===
2026-05-28 15:38:05,760 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-28 15:38:05,760 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-28 15:38:05,803 [INFO] predictor: Models loaded OK
2026-05-28 15:38:17,383 [INFO] scraper: odds3t: 120/120 parsed
2026-05-28 15:38:18,496 [INFO] scraper: odds3f: 20/20 parsed
2026-05-28 15:38:19,697 [INFO] scraper: odds2t: 28/30 parsed
2026-05-28 15:38:19,698 [INFO] scraper: odds2f: 15/15 parsed
2026-05-28 15:38:20,811 [INFO] scraper: odds_win: 4/6 parsed
2026-05-28 15:38:20,811 [INFO] scraper: fetch_race 15/2: boats=6 odds=187/191
2026-05-28 15:38:20,824 [INFO] predictor: CALIBRATION_MODE=on
2026-05-28 15:38:20,824 [INFO] predictor: combos: {'win': 4, '2t': 28, '3t': 120}
2026-05-28 15:38:20,831 [INFO] run_cycle: fetched 15/2 [scan]: 152 combos
2026-05-28 15:38:20,929 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-28 15:39:05,640 [INFO] run_cycle: === run_cycle 15:39:05 ===
2026-05-28 15:39:05,640 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-28 15:39:05,640 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-28 15:39:05,709 [INFO] predictor: Models loaded OK
2026-05-28 15:39:06,136 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 62
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 62
  }
]
```

## Phase別通知記録 (24h)
{'final': 26, 'result': 10, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 45
  FINAL_MISSING: 42
  PSI_DRIFT_DETECTED: 36
  CIRCUIT_BREAKER_TRIP: 21
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 12
  ANOMALY_SCAN_FINAL_RATIO: 6
  KS_ODDS_DRIFT: 6
  LARGE_ODDS_DRIFT: 2
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 30 | 7 | 9,000 | 8,010 | -990 | 0.89 |
| S01_NAKAANA1 | 30 | 6 | 6,000 | 3,640 | -2,360 | 0.607 |
| S02_TETSUBAN | 14 | 9 | 2,800 | 3,540 | +740 | 1.264 |

## 直近アラート (24h・新しい順)
```
[15:35:34] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.004663, "ks_stat": 0.227}
[15:35:34] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 240, "n_recent": 74, "psi": 0.551}
[15:21:29] CIRCUIT_BREAKER_TRIP: {"cost": 6000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 30, "payout": 3640, "roi_7d": 0.607, "sid": "S01_NAKAANA1"}
[15:21:29] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.003694, "ks_stat": 0.231}
[15:21:29] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 239, "n_recent": 75, "psi": 0.545}
[15:21:29] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": 22.5, "final": 4.9, "kind": "LARGE_ODDS_DRIFT", "race": "011R", "scan": 4.0, "sid": "S01_NAKAANA1"}
[15:17:37] FINAL_MISSING: {"deadline": "2026-05-28T10:46:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052818061046", "sid": "S00"}
[15:06:05] FINAL_MISSING: {"deadline": "2026-05-28T14:36:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052817081436", "sid": "S00"}
[15:04:34] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:04:34] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 53件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 91件 締切済
- 通知発射: scan=15 nid / final=17 nid / result=7 nid
- predictions: 9 / うち結果DB記録済: 7
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 011R | win | 1 | 0.4111 | 4.9 | 2.01 | 200 | scan=4.0 drift=+22.5% | 15:21:21 |
| S00 | 011R | win | 1 | 0.4111 | 4.9 | 2.01 | 300 | scan=4.0 drift=+22.5% | 15:21:21 |
| S02_TETSUBAN | 039R | win | 1 | 0.5735 | 2.3 | 1.32 | 200 | scan=- drift=- | 14:49:32 |
| S01_NAKAANA1 | 029R | win | 1 | 0.5123 | 3.7 | 1.90 | 200 | scan=- drift=- | 14:45:23 |
| S01_NAKAANA1 | 178R | win | 1 | 0.5123 | 4.2 | 2.15 | 200 | scan=4.0 drift=+5.0% | 14:33:32 |
| S00 | 027R | win | 1 | 0.5334 | 5.3 | 2.83 | 300 | scan=28.5 drift=-81.4% | 13:42:32 |
| S01_NAKAANA1 | 088R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=- drift=- | 13:41:22 |
| S00 | 108R | win | 1 | 0.3177 | 5.0 | 1.59 | 300 | scan=- drift=- | 11:49:31 |
| S02_TETSUBAN | 031R | win | 1 | 0.5735 | 2.3 | 1.32 | 200 | scan=- drift=- | 11:11:20 |
| S00 | 074R | win | 1 | 0.4111 | 5.7 | 2.34 | 300 | scan=- drift=- | 17:15:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 42 | -3.0% | -81.4% | +157.5% | 16 | 9 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 518.3s |
| **Latency** (scan→final max) | 611.8s |
| **Traffic** (notifications 24h) | 62 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 312 | 0.4543 | 0.3205 | +0.1338 | 🟡+29% | 0.2353 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 175 | 0.4233 | 0.2857 | 0.2229 | 🔴-0.09 | 0.969 |
| S01_NAKAANA1 | win | 86 | 0.4837 | 0.2907 | 0.2486 | 🔴-0.21 | 0.801 |
| S02_TETSUBAN | win | 51 | 0.5110 | 0.4902 | 0.2555 | 🔴-0.02 | 0.933 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.15-0.20 | 5 | 0.1957 | 0.2000 | ✅-0.0043 |
| 0.20-0.30 | 12 | 0.2234 | 0.4167 | 🔴-0.1933 |
| 0.30-0.50 | 139 | 0.4171 | 0.2878 | 🔴+0.1293 |
| 0.50+ | 147 | 0.5400 | 0.3673 | 🔴+0.1726 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 25 | 0.783 |
| win | <5.0 | ✅learned | 41 | 0.83 |
| win | <10.0 | ✅learned | 37 | 0.538 |
| win | <20.0 | ✅learned | 11 | 0.193 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-05-28T15:40:02.154872+09:00_
# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-19T11:50:02.049040+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×23 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×35 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×23 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×46  [2026-05-19T11:02:21]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×46  [2026-05-19T11:02:21]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×46  [2026-05-19T11:02:21]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×46  [2026-05-19T11:02:21]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-05-19T11:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×18  [2026-05-19T10:47:47]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×15  [2026-05-19T10:00:26]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-19T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1907 actual=0.1429 gap=+0.0479`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-19T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=44 hit%=25.0% ROI=0.66 (コスト 13,000/回収 8,550)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-19T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=14 pred=0.0049 actual=0.0714 gap=-0.0665`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-19T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=193<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-19T06:00:11]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=20 hit%=35.0% ROI=1.00 (コスト 5,400/回収 5,400)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-19T06:00:11]
- key: `DRIFT_BUCKET|drift ≥+30%: n=35 hit%=22.9% ROI=0.66 (コスト 9,200/回収 6,080)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-19T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=11 pred=0.2239 actual=0.3636 gap=-0.1397`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-19T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=21 pred=0.3263 actual=0.1429 gap=+0.1835`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-19T06:00:11]
- key: `ROI_STAT|S00: n=193 hit%=26.4% hit_CI[Bonf]=[18.4,36.4]% ROI=0.87 ROI_boot95=[0.63,1.12]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-19T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=46 hit%=32.6% hit_CI[Bonf]=[16.7,53.8]% ROI=0.70 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-19T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=46<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-19T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=32 hit%=46.9% hit_CI[Bonf]=[24.8,70.2]% ROI=0.90 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-19T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=32<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 2.95MB / last modified 2026-05-19T11:49:45.349400+09:00

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
&hd=20260519: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-05-19 11:49:27,894 [INFO] scraper: odds3t: 120/120 parsed
2026-05-19 11:49:28,978 [INFO] scraper: odds3f: 20/20 parsed
2026-05-19 11:49:30,059 [INFO] scraper: odds2t: 30/30 parsed
2026-05-19 11:49:30,060 [INFO] scraper: odds2f: 15/15 parsed
2026-05-19 11:49:31,150 [INFO] scraper: odds_win: 6/6 parsed
2026-05-19 11:49:31,150 [INFO] scraper: fetch_race 08/4: boats=6 odds=191/191
2026-05-19 11:49:31,161 [INFO] predictor: CALIBRATION_MODE=on
2026-05-19 11:49:31,162 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-19 11:49:31,169 [INFO] run_cycle: fetched 08/4 [final]: 156 combos
2026-05-19 11:49:34,627 [INFO] scraper: odds3t: 120/120 parsed
2026-05-19 11:49:35,712 [INFO] scraper: odds3f: 20/20 parsed
2026-05-19 11:49:36,820 [INFO] scraper: odds2t: 27/30 parsed
2026-05-19 11:49:36,821 [INFO] scraper: odds2f: 15/15 parsed
2026-05-19 11:49:37,909 [INFO] scraper: odds_win: 2/6 parsed
2026-05-19 11:49:37,909 [INFO] scraper: fetch_race 16/3: boats=6 odds=184/191
2026-05-19 11:49:37,919 [INFO] predictor: CALIBRATION_MODE=on
2026-05-19 11:49:37,921 [INFO] predictor: combos: {'win': 2, '2t': 27, '3t': 120}
2026-05-19 11:49:37,927 [INFO] run_cycle: fetched 16/3 [scan]: 149 combos
2026-05-19 11:49:41,459 [INFO] scraper: odds3t: 120/120 parsed
2026-05-19 11:49:42,536 [INFO] scraper: odds3f: 20/20 parsed
2026-05-19 11:49:43,612 [INFO] scraper: odds2t: 30/30 parsed
2026-05-19 11:49:43,613 [INFO] scraper: odds2f: 15/15 parsed
2026-05-19 11:49:44,740 [INFO] scraper: odds_win: 6/6 parsed
2026-05-19 11:49:44,741 [INFO] scraper: fetch_race 18/8: boats=6 odds=191/191
2026-05-19 11:49:44,750 [INFO] predictor: CALIBRATION_MODE=on
2026-05-19 11:49:44,842 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-19 11:49:44,846 [INFO] run_cycle: fetched 18/8 [scan]: 156 combos
2026-05-19 11:49:44,948 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 36
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 36
  }
]
```

## Phase別通知記録 (24h)
{'final': 13, 'result': 6, 'scan': 17}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 69
  KS_ODDS_DRIFT: 37
  FINAL_MISSING: 35
  CIRCUIT_BREAKER_TRIP: 23
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 7
  ANOMALY_BET_VOLUME_DROP: 3
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 11 | 10,800 | 9,240 | -1,560 | 0.856 |
| S01_NAKAANA1 | 32 | 9 | 6,400 | 3,880 | -2,520 | 0.606 |
| S02_TETSUBAN | 19 | 9 | 3,800 | 3,100 | -700 | 0.816 |

## 直近アラート (24h・新しい順)
```
[11:49:44] CIRCUIT_BREAKER_TRIP: {"cost": 6400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 32, "payout": 3880, "roi_7d": 0.606, "sid": "S01_NAKAANA1"}
[11:49:44] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.442}
[11:49:44] FINAL_MISSING: {"deadline": "2026-05-19T10:18:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051914051018", "sid": "S00"}
[11:46:32] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.448}
[11:46:32] FINAL_MISSING: {"deadline": "2026-05-19T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051902021116", "sid": "S00"}
[11:17:30] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.455}
[11:17:30] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": -22.6, "final": 10.6, "kind": "LARGE_ODDS_DRIFT", "race": "147R", "scan": 13.7, "sid": "S00"}
[11:17:30] FINAL_MISSING: {"deadline": "2026-05-19T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051902011047", "sid": "S00"}
[11:13:44] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.464}
[11:11:36] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.272, "baseline_mean": 0.772, "baseline_stdev": 0.065, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 6, "z_score": -4.21}
```

## 本日残レース: 102件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 30件 締切済
- 通知発射: scan=6 nid / final=4 nid / result=2 nid
- predictions: 3 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 147R | win | 1 | 0.4111 | 10.6 | 4.36 | 300 | scan=13.7 drift=-22.6% | 11:17:21 |
| S01_NAKAANA1 | 082R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=3.2 drift=+12.5% | 10:54:32 |
| S01_NAKAANA1 | 145R | win | 1 | 0.4989 | 4.2 | 2.10 | 200 | scan=4.0 drift=+5.0% | 10:15:21 |
| S02_TETSUBAN | 2012R | win | 1 | 0.5334 | 2.2 | 1.17 | 200 | scan=2.2 drift=+0.0% | 22:51:33 |
| S01_NAKAANA1 | 153R | win | 1 | 0.5123 | 3.8 | 1.95 | 200 | scan=- drift=- | 16:31:45 |
| S02_TETSUBAN | 215R | win | 1 | 0.5735 | 2.3 | 1.32 | 200 | scan=2.6 drift=-11.5% | 12:35:22 |
| S01_NAKAANA1 | 149R | win | 1 | 0.5334 | 3.7 | 1.97 | 200 | scan=- drift=- | 12:23:22 |
| S00 | 142R | win | 1 | 0.4111 | 8.8 | 3.62 | 300 | scan=- drift=- | 09:03:21 |
| S02_TETSUBAN | 209R | win | 1 | 0.5334 | 2.5 | 1.33 | 200 | scan=2.4 drift=+4.2% | 21:25:22 |
| S00 | 155R | win | 1 | 0.2290 | 11.6 | 2.66 | 300 | scan=- drift=- | 17:34:32 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 54 | +8.4% | -76.3% | +522.0% | 18 | 8 | 34 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 476.4s |
| **Latency** (scan→final max) | 602.4s |
| **Traffic** (notifications 24h) | 36 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 273 | 0.4538 | 0.2967 | +0.1571 | 🟡+35% | 0.2314 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 193 | 0.4355 | 0.2642 | 0.2273 | 🔴-0.17 | 0.869 |
| S01_NAKAANA1 | win | 48 | 0.4909 | 0.3125 | 0.2353 | 🔴-0.10 | 0.669 |
| S02_TETSUBAN | win | 32 | 0.5085 | 0.4688 | 0.2502 | 🔴-0.00 | 0.897 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 14 | 0.0049 | 0.0714 | 🔴-0.0665 |
| 0.15-0.20 | 7 | 0.1907 | 0.1429 | ✅+0.0479 |
| 0.20-0.30 | 11 | 0.2239 | 0.3636 | 🔴-0.1397 |
| 0.30-0.50 | 123 | 0.4251 | 0.2439 | 🔴+0.1812 |
| 0.50+ | 124 | 0.5406 | 0.3629 | 🔴+0.1777 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 15 | 0.795 |
| win | <5.0 | ✅learned | 29 | 0.715 |
| win | <10.0 | ✅learned | 26 | 0.556 |
| win | <20.0 | ✅learned | 11 | 0.193 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-05-19T11:50:02.049040+09:00_
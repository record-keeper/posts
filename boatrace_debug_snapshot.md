# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-12T13:10:01.836501+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🔴 PSI_DRIFT_DETECTED×36 (24h)
- 🟡 FINAL_MISSING×34 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×8  [2026-05-12T13:02:47]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×8  [2026-05-12T13:02:47]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×8  [2026-05-12T13:02:47]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×1  [2026-05-12T12:05:30]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-12T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2241 actual=0.3333 gap=-0.1093`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-12T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1899 actual=0.1667 gap=+0.0232`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-12T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=13 pred=0.0030 actual=0.0769 gap=-0.0739`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-12T06:00:08]
- key: `ROI_STAT|S00: n=157 hit%=25.5% hit_CI[Bonf]=[16.9,36.6]% ROI=0.87 ROI_boot95=[0.61,1.16]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-12T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S00: n=157<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-12T06:00:08]
- key: `ORPHAN_SCAN|195 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-12T06:00:08]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=17.1% ROI=0.44 (コスト 10,300/回収 4,560)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-12T06:00:08]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=26 hit%=30.8% ROI=1.52 (コスト 6,400/回収 9,720)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-12T06:00:08]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=34 hit%=29.4% ROI=1.17 (コスト 8,700/回収 10,170)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-12T06:00:08]
- key: `DRIFT_BUCKET|drift ≥+30%: n=27 hit%=22.2% ROI=0.64 (コスト 7,200/回収 4,600)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-12T06:00:08]
- key: `CALIBRATION_LIVE|bt=win: n=184 pred=0.4449 actual=0.2772 error=+0.1677 (+38%) brier=0.2331 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-12T06:00:08]
- key: `CALIBRATION_LIVE|S00(win): n=157 pred=0.4363 hit=0.2548 cal_err=+0.1816 brier=0.2298 BSS=-0.21 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-12T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=16 pred=0.3290 actual=0.1875 gap=+0.1415`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-12T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=72 pred=0.4463 actual=0.2639 gap=+0.1824`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-12T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.50+: n=76 pred=0.5376 actual=0.3158 gap=+0.2218`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-12T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 2.57MB / last modified 2026-05-12T13:09:35.274611+09:00

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
by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-12 13:09:06,240 [INFO] predictor: Models loaded OK
2026-05-12 13:09:17,745 [INFO] scraper: odds3t: 120/120 parsed
2026-05-12 13:09:18,856 [INFO] scraper: odds3f: 20/20 parsed
2026-05-12 13:09:20,025 [INFO] scraper: odds2t: 30/30 parsed
2026-05-12 13:09:20,027 [INFO] scraper: odds2f: 15/15 parsed
2026-05-12 13:09:21,120 [INFO] scraper: odds_win: 5/6 parsed
2026-05-12 13:09:21,120 [INFO] scraper: fetch_race 03/6: boats=6 odds=190/191
2026-05-12 13:09:21,133 [INFO] predictor: CALIBRATION_MODE=on
2026-05-12 13:09:21,133 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-05-12 13:09:21,140 [INFO] run_cycle: fetched 03/6 [final]: 155 combos
2026-05-12 13:09:24,785 [INFO] scraper: odds3t: 120/120 parsed
2026-05-12 13:09:25,884 [INFO] scraper: odds3f: 20/20 parsed
2026-05-12 13:09:27,021 [INFO] scraper: odds2t: 28/30 parsed
2026-05-12 13:09:27,022 [INFO] scraper: odds2f: 12/15 parsed
2026-05-12 13:09:28,119 [INFO] scraper: odds_win: 2/6 parsed
2026-05-12 13:09:28,121 [INFO] scraper: fetch_race 08/7: boats=6 odds=182/191
2026-05-12 13:09:28,136 [INFO] predictor: CALIBRATION_MODE=on
2026-05-12 13:09:28,136 [INFO] predictor: combos: {'win': 2, '2t': 28, '3t': 120}
2026-05-12 13:09:28,148 [INFO] run_cycle: fetched 08/7 [scan]: 150 combos
2026-05-12 13:09:31,785 [INFO] scraper: odds3t: 120/120 parsed
2026-05-12 13:09:32,861 [INFO] scraper: odds3f: 20/20 parsed
2026-05-12 13:09:33,942 [INFO] scraper: odds2t: 24/30 parsed
2026-05-12 13:09:33,943 [INFO] scraper: odds2f: 10/15 parsed
2026-05-12 13:09:35,091 [INFO] scraper: odds_win: 3/6 parsed
2026-05-12 13:09:35,091 [INFO] scraper: fetch_race 11/7: boats=6 odds=177/191
2026-05-12 13:09:35,101 [INFO] predictor: CALIBRATION_MODE=on
2026-05-12 13:09:35,101 [INFO] predictor: combos: {'win': 3, '2t': 24, '3t': 120}
2026-05-12 13:09:35,109 [INFO] run_cycle: fetched 11/7 [scan]: 147 combos
2026-05-12 13:09:35,220 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 72
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 72
  }
]
```

## Phase別通知記録 (24h)
{'final': 27, 'result': 18, 'scan': 27}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 85
  PSI_DRIFT_DETECTED: 36
  KS_ODDS_DRIFT: 35
  FINAL_MISSING: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 7
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 14 | 12,600 | 12,360 | -240 | 0.981 |
| S01_NAKAANA1 | 16 | 6 | 3,200 | 2,540 | -660 | 0.794 |
| S02_TETSUBAN | 14 | 7 | 2,800 | 2,880 | +80 | 1.029 |
| S04_SELL_3T | 12 | 1 | 1,200 | 740 | -460 | 0.617 |

## 直近アラート (24h・新しい順)
```
[13:04:21] FINAL_MISSING: {"deadline": "2026-05-12T12:34:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051222011234", "sid": "S00"}
[13:02:46] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:01:32] FINAL_MISSING: {"deadline": "2026-05-12T12:31:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051216041231", "sid": "S00"}
[12:59:36] FINAL_MISSING: {"deadline": "2026-05-12T11:29:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051211031129", "sid": "S00"}
[12:47:22] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 2e-06, "ks_stat": 0.387}
[12:47:22] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 118, "n_recent": 72, "psi": 0.338}
[12:28:28] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.403}
[12:28:28] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 117, "n_recent": 73, "psi": 0.335}
[12:16:27] FINAL_MISSING: {"deadline": "2026-05-12T11:46:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051223081146", "sid": "S00"}
[12:12:23] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 1e-06, "ks_stat": 0.395}
```

## 本日残レース: 105件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 63件 締切済
- 通知発射: scan=14 nid / final=13 nid / result=6 nid
- predictions: 6 / うち結果DB記録済: 6
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 034R | win | 1 | 0.5174 | 2.6 | 1.35 | 200 | scan=2.2 drift=+18.2% | 12:12:21 |
| S01_NAKAANA1 | 084R | win | 1 | 0.4989 | 3.3 | 1.65 | 200 | scan=3.0 drift=+10.0% | 11:48:20 |
| S00 | 033R | win | 1 | 0.1957 | 4.7 | 0.92 | 300 | scan=14.2 drift=-66.9% | 11:46:21 |
| S00 | 237R | win | 1 | 0.5123 | 6.5 | 3.33 | 300 | scan=- drift=- | 11:13:21 |
| S01_NAKAANA1 | 111R | win | 1 | 0.5735 | 3.6 | 2.06 | 200 | scan=- drift=- | 10:31:20 |
| S00 | 142R | win | 1 | 0.2173 | 6.7 | 1.46 | 300 | scan=- drift=- | 09:11:31 |
| S02_TETSUBAN | 208R | win | 1 | 0.5735 | 2.8 | 1.61 | 200 | scan=- drift=- | 18:30:25 |
| S01_NAKAANA1 | 204R | win | 1 | 0.4989 | 3.7 | 1.85 | 200 | scan=4.1 drift=-9.8% | 16:37:46 |
| S01_NAKAANA1 | 229R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=3.2 drift=+9.4% | 16:20:25 |
| S02_TETSUBAN | 1112R | win | 1 | 0.4480 | 2.0 | 0.90 | 200 | scan=- drift=- | 16:13:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| 3t | 12 | +11.6% | -41.4% | +75.7% | 5 | 1 | 9 |
| win | 51 | -8.2% | -75.4% | +124.4% | 25 | 16 | 37 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 455.2s |
| **Latency** (scan→final max) | 624.3s |
| **Traffic** (notifications 24h) | 72 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 190 | 0.4441 | 0.2789 | +0.1651 | 🟡+37% | 0.2311 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 160 | 0.4339 | 0.2500 | 0.2277 | 🔴-0.21 | 0.856 |
| S01_NAKAANA1 | win | 16 | 0.4998 | 0.3750 | 0.2356 | 🔴-0.01 | 0.794 |
| S02_TETSUBAN | win | 14 | 0.4965 | 0.5000 | 0.2647 | 🔴-0.06 | 1.029 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 13 | 0.0030 | 0.0769 | 🔴-0.0739 |
| 0.15-0.20 | 7 | 0.1907 | 0.1429 | ✅+0.0479 |
| 0.20-0.30 | 10 | 0.2234 | 0.3000 | 🔴-0.0766 |
| 0.30-0.50 | 89 | 0.4258 | 0.2472 | 🔴+0.1786 |
| 0.50+ | 79 | 0.5374 | 0.3291 | 🔴+0.2083 |

## Settlement Ratio データ品質

- 学習済み: 2バンド / fallback: 15バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 7 | 0.4 |
| win | <5.0 | ✅learned | 13 | 0.876 |
| win | <10.0 | ✅learned | 25 | 0.564 |
| win | <20.0 | ⚠️fallback | 8 | 0.22 |
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
_auto-generated by claude_snapshot.py at 2026-05-12T13:10:01.836501+09:00_